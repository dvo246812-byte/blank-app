
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

# 1. Cau hinh trang web
st.set_page_config(
    page_title="Quan ly diem sinh vien",
    layout="wide"
)

# 2. Tao tieu de
st.title("QUAN LY DIEM SINH VIEN")
st.write("Ung dung quan ly, thong ke va xep loai diem.")

# 3. Tao du lieu 10 sinh vien
data = {
    "MSSV": [
        "SV001", "SV002", "SV003", "SV004", "SV005",
        "SV006", "SV007", "SV008", "SV009", "SV010"
    ],
    "Ho ten": [
        "An", "Binh", "Chi", "Dung", "Ha",
        "Hung", "Lan", "Minh", "Nam", "Phuong"
    ],
    "Chuyen can": [8, 9, 7, 10, 8, 6, 9, 7, 8, 10],
    "Giua ky":    [7, 8, 6, 9, 7, 5, 8, 7, 6, 9],
    "Cuoi ky":    [9, 8, 7, 10, 8, 6, 9, 8, 7, 10]
}

df = pd.DataFrame(data)

# 4. Tinh diem tong ket
df["Tong ket"] = (
    0.2 * df["Chuyen can"]
    + 0.3 * df["Giua ky"]
    + 0.5 * df["Cuoi ky"]
)

# 5. Xep loai sinh vien
def xep_loai(diem):
    if diem >= 8.5:
        return "Gioi"
    elif diem >= 7.0:
        return "Kha"
    elif diem >= 5.0:
        return "Trung binh"
    else:
        return "Yeu"

df["Xep loai"] = df["Tong ket"].apply(xep_loai)

# 6. Hien thi bang diem
st.subheader("1. Bang diem 10 sinh vien")
st.dataframe(df, use_container_width=True)

# 7. Thong ke
st.subheader("2. Thong ke ket qua hoc tap")

diem_tb = df["Tong ket"].mean()
cao_nhat = df["Tong ket"].max()
thap_nhat = df["Tong ket"].min()
so_dat = (df["Tong ket"] >= 5).sum()

sv_cao = df[df["Tong ket"] == cao_nhat]
sv_thap = df[df["Tong ket"] == thap_nhat]

c1, c2, c3 = st.columns(3)

c1.metric("Diem trung binh", f"{diem_tb:.2f}")
c2.metric("Diem cao nhat", f"{cao_nhat:.2f}")
c3.metric("So sinh vien dat", f"{so_dat}/10")

st.write("**Sinh vien co diem cao nhat:**")
st.dataframe(sv_cao, use_container_width=True)

st.write("**Sinh vien co diem thap nhat:**")
st.dataframe(sv_thap, use_container_width=True)

# 8. Chon sinh vien bang Selectbox
st.subheader("3. Tra cuu diem sinh vien")

ten_sv = st.selectbox(
    "Chon mot sinh vien:",
    df["Ho ten"].tolist()
)

sv = df[df["Ho ten"] == ten_sv].iloc[0]

st.write("**Ho ten:**", sv["Ho ten"])
st.write("**MSSV:**", sv["MSSV"])
st.write("**Diem chuyen can:**", sv["Chuyen can"])
st.write("**Diem giua ky:**", sv["Giua ky"])
st.write("**Diem cuoi ky:**", sv["Cuoi ky"])
st.write("**Diem tong ket:**", f'{sv["Tong ket"]:.2f}')
st.write("**Xep loai:**", sv["Xep loai"])

# 9. Ve bieu do
st.subheader("4. Bieu do diem tong ket")

fig, ax = plt.subplots(figsize=(10, 5))

ax.bar(df["Ho ten"], df["Tong ket"])
ax.set_title("DIEM TONG KET CUA 10 SINH VIEN")
ax.set_xlabel("Ho ten sinh vien")
ax.set_ylabel("Diem tong ket")
ax.set_ylim(0, 10)

plt.xticks(rotation=45)
fig.tight_layout()

st.pyplot(fig)
plt.close(fig)

# 10. Thong tin nguoi tao
st.divider()
st.caption("Nguoi tao: [Võ Trung Đạt] - MSSV: [060208003897]")
